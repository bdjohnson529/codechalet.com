---
layout: blog
title:  "Virtual Environments"
order: 2
topic: Python
topic_path: /docs/python/index.html
---
Create a venv
```bash
python -m venv venv
```

Activate venv
```bash
source venv/bin/activate
```

## Project Dependencies

Install packages from a file
```bash
pip install -r requirements.txt
```

Update requirements file
```bash
python -m pip freeze > requirements.txt
```