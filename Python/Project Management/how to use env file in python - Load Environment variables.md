---
title: how to use .env file in python | Load Environment Variables from .env file
created: 2026-06-04
tags:
  - commands
  - best-practices
  - advanced
  - tools
aliases:
  - env
  - environment
---
![https://youtu.be/8dlQ_nDE7dQ?si=tWu1B9vqNF9ApvJ7](https://youtu.be/8dlQ_nDE7dQ?si=tWu1B9vqNF9ApvJ7)

[How to Use Python Environment Variables](https://www.youtube.com/watch?v=sOwG0bw0RNU)

[How to use a .env file to load environment variables in a dev container](https://www.youtube.com/watch?v=qTU7w3bWrOk)

[What are Environment Variables | Hacking?](https://www.youtube.com/watch?v=KjZ3IakXzFA)

[What are Environment Variables, and how do I use them? (get,set)](https://www.youtube.com/watch?v=ADh_OFBfdEE)

```text
How to access .env file contents in Python? Why is it necessary? Is the .env file safe to store credentials and then access them through the OS module?
```

**The most common approach is using the `python-dotenv` library**, which reads environment variables from a `.env` file and loads them into your application.

```bash
### Using python-dotenv

# First, install the library:

uv add python-dotenv
```

Then, create a `.env` file in your project root:

```
DATABASE_URL=postgresql://user:password@localhost/mydb
API_KEY=your_secret_api_key_here
DEBUG=True
```

Access the variables in your Python code:

```python
import os
from dotenv import load_dotenv

# Load variables from .env file
load_dotenv()

# Access environment variables
database_url = os.getenv('DATABASE_URL')
api_key = os.getenv('API_KEY')
debug_mode = os.getenv('DEBUG', 'False')  # Default value if not found
```

#### Using os.environ directly

You can also access environment variables without `python-dotenv` if they're already set in your system:

```python
import os

api_key = os.environ.get('API_KEY')  # Returns None if not found
db_password = os.environ['DB_PASSWORD']  # Raises KeyError if not found
```

### Why .env Files Are Necessary

- **Separation of configuration from code:** Environment variables allow you to change configuration without modifying source code. This is essential for using different settings across development, testing, and production environments.
- **Security:** Credentials shouldn't be hardcoded in your codebase where they're committed to version control and visible to anyone with repository access.
- **Local development:** Developers can have their own `.env` files with local database credentials, API keys, and settings without affecting others.
- **Easy deployment:** When deploying to production servers, cloud platforms, or Docker containers, you simply set environment variables differently without changing your code.

## Is .env Safe for Credentials?

- *The short answer: A .env file itself is NOT inherently safe, but it's a practical compromise when used correctly.**

### The Risks

- *Version control exposure:** If you accidentally commit `.env` to Git, your credentials are exposed in your repository history permanently. Even if you delete it later, it remains in the Git history.
- *File system access:** Anyone with filesystem access to your server can read the `.env` file if permissions aren't configured correctly.
- *Less secure than dedicated systems:** .env files are plain text—they're not encrypted and don't provide the security of dedicated secret management systems.

### How to Use It Safely

**Add .env to `.gitignore`:** This is the critical step.

```bash
# .gitignore
.env
.env.local
*.env
```

**Set proper file permissions:** On Linux/Mac, restrict read access:

```bash
chmod 600 .env
```

**Never commit sample files with real secrets:** Use `.env.example` with placeholder values:

```
# .env.example
DATABASE_URL=your_database_url_here
API_KEY=your_api_key_here
```

- ***For production, use dedicated services:**** Instead of .env files on production servers, use:
- ****AWS Secrets Manager**** or ****AWS Systems Manager Parameter Store****
- ****Google Cloud Secret Manager****
- ****Azure Key Vault****
- ****HashiCorp Vault****
- ****Kubernetes Secrets**** (if using containers)

### **Using `os.environ` with `.env` is safe because:**

- The OS module simply reads environment variables into your application memory—it doesn't create additional security vulnerabilities
- Environment variables don't get logged or printed accidentally like hardcoded strings might
- They're isolated from your codebase and can be rotated without code changes
- *Bottom line:** .env files are acceptable for **local development**, but for **production systems**, use dedicated secret management tools that provide encryption, access control, rotation, and audit logging.

```
Can U please explain more about the .env.example` file? You mentioned above
```

**A `.env.example` file is a template that shows which environment variables your application needs, without containing any actual sensitive values.** It serves as documentation and a setup guide for developers.

### Why It's Necessary

- *Onboarding new developers:** When someone clones your project, they immediately see which environment variables they need to configure. Without it, they have to search through the code to discover what's required.
- *Documentation:** It acts as living documentation of your application's configuration requirements.
- *Safe to commit:** Since it contains no real secrets, you can safely add it to version control (Git) so the entire team has it.
- *Prevents broken setups:** New developers won't accidentally miss required variables and spend time debugging cryptic errors.

## Example: Comparing `.env` vs `.env.example`

### Your actual `.env` file (never committed):

```
DATABASE_URL=postgresql://john:secretpassword123@localhost:5432/myapp_db
API_KEY=sk_live_abc123xyz789def456ghi789jkl
JWT_SECRET=my_super_secret_jwt_key_dont_share
STRIPE_SECRET_KEY=sk_test_51IqZ8K2eZvLpCk4X9Q9X9Q9X
EMAIL_PASSWORD=gmail_app_password_here
DEBUG=False
LOG_LEVEL=info
```

### Your `.env.example` file (committed to Git):

```
DATABASE_URL=postgresql://username:password@localhost:5432/database_name
API_KEY=your_api_key_here
JWT_SECRET=your_jwt_secret_here
STRIPE_SECRET_KEY=your_stripe_key_here
EMAIL_PASSWORD=your_email_password_here
DEBUG=False
LOG_LEVEL=info
```

## How to Create and Use It

### Step 1: Create the template

Copy your `.env` file and remove all sensitive values, replacing them with descriptive placeholders:

```bash
# Create from existing .env
cp .env .env.example

# Or create manually
touch .env.example
```

### Step 2: Edit with placeholders

Replace real values with descriptions of what should go there:

```
# Database configuration
DATABASE_URL=postgresql://username:password@host:port/dbname

# API credentials
OPENAI_API_KEY=sk_xxxx...
GITHUB_TOKEN=ghp_xxxx...

# Service keys
STRIPE_PUBLIC_KEY=pk_live_xxxx...
STRIPE_SECRET_KEY=sk_live_xxxx...

# Application settings
DEBUG=True
PORT=3000
ENVIRONMENT=development
```

### Step 3: Add to version control

```bash
# .gitignore
.env
.env.local

# .env.example is NOT in .gitignore—it gets committed
```

### Step 4: New developers use it

When someone clones your repo:

```bash
# Clone the repository
git clone <repo-url>

# Copy the example file as their working .env
cp .env.example .env

# Edit with their actual values
nano .env
```

---

## Best Practices

**Use descriptive placeholder names:** Instead of `STRIPE_KEY=xxx`, use `STRIPE_SECRET_KEY=sk_live_your_live_secret_key_here` so developers know exactly what format is expected.

**Group related variables:** Organise by service or functionality for clarity.

```
# Database
DATABASE_URL=...
DATABASE_POOL_SIZE=...

# AWS
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...

# Email
SMTP_HOST=...
SMTP_PORT=...
SMTP_USER=...
```

**Include comments explaining required variables:**

```
# Required: Your OpenAI API key from <https://platform.openai.com/api-keys>
OPENAI_API_KEY=sk_xxxx...

# Optional: Enable verbose logging (default: False)
DEBUG=False
```

**Specify data types and formats:**

```
# Must be a valid PostgreSQL connection string
DATABASE_URL=postgresql://user:pass@host:5432/db

# Must be an integer between 1 and 100
MAX_WORKERS=10

# Boolean value: True or False
ENABLE_CACHING=True
```

**Keep it updated:** Whenever you add new environment variables to your application, immediately add them to `.env.example`. This prevents it from getting out of sync.

---

## Common Patterns

Some teams use different naming conventions:

```
.env.example          # Template for all environments
.env.development      # Committed example for development
.env.production       # Committed example for production (no secrets!)
.env.test            # Committed example for testing
```

This way, each environment has documentation of what variables it needs, and developers can understand differences between environments.