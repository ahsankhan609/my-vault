---
created: 2026-06-03
published: 2026-03-27
course-url: https://www.youtube.com/playlist?list=PLEt8Tae2spYnHy378vMlPH--87cfeh33P
course-github: https://github.com/jod35/fastapi-beyond-CRUD
fast-api docs: https://fastapi.tiangolo.com/
HTTP client: https://restfox.dev/
---
Fast API is a famous [[web-framework]] for building web apps using the Python programming Language.

### setting up project

```bash
uv init project_name --python 3.14.5
```

```bash
uv add fastapi uvicorn
```

```bash
uv add --dev pytest ruff
```

**boiler plate:**

```python
@app.get("/")

def read_root() -> dict[str, str]:

    """Root endpoint."""

    return {"message": "Hello World"}
```

```python
@app.get("/health")

async def health() -> dict[str, str]:

    """Health endpoint."""

    return {"status": "ok"}
```

### running project

run `app` in `development mode`

```bash
fasapi dev 
```

run `app` in `Production mode`

```bash
fastpi run
```

### choosing a HTTP client
in a real world scenario, we use a HTTP client to test these different methods (get, post, delete, PUT, PATCH, DELETE, HEAD) requests.
there are many clients such as `Postman`, `Insomnia` etc... But will use `REST Fox` because it is lightweight and open source tool for making these HTTP requests.
https://restfox.dev/

![Add new workspace for project](../Attachments/Pasted%20image%2020260603203541.png)

![Add new Request](../Attachments/Pasted%20image%2020260603203757.png)

![test endpoint with path-parameter](../Attachments/Pasted%20image%2020260603204646.png)

![test endpoint with query parameter](../Attachments/Pasted%20image%2020260603205738.png)

![mixing path-query-parameter](../Attachments/Pasted%20image%2020260603210522.png)
