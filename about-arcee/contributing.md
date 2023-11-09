# Contributing

## [Contributing](https://github.com/arcee-ai/arcee-python#contributing) <a href="#user-content-contributing" id="user-content-contributing"></a>

We use `invoke` to manage this repo. You don't need to use it, but it simplifies the workflow.

### [Set up the repo](https://github.com/arcee-ai/arcee-python#set-up-the-repo) <a href="#user-content-set-up-the-repo" id="user-content-set-up-the-repo"></a>

```
git clone https://github.com/arcee-ai/arcee-python && cd arcee-python
# optionally setup your virtual environment (recommended)
python -m venv .venv && source .venv/bin/activate
# install repo
pip install invoke
inv install
```

### [Format, lint, test](https://github.com/arcee-ai/arcee-python#format-lint-test) <a href="#user-content-format-lint-test" id="user-content-format-lint-test"></a>

```
inv format  # run black and ruff
inv lint    # black check, ruff check, mypy
inv test    # pytest
```

### [Publishing](https://github.com/arcee-ai/arcee-python#publishing) <a href="#user-content-publishing" id="user-content-publishing"></a>

We publish in this repo by creating a new release/tag in github. On release, a github action will publish the `__version__` of arcee-py that is in `arcee/__init__.py`

**So you need to increase that version before releasing, otherwise it will fail**

#### [To create a new release](https://github.com/arcee-ai/arcee-python#to-create-a-new-release) <a href="#user-content-to-create-a-new-release" id="user-content-to-create-a-new-release"></a>

1. Open a PR increasing the `__version__` of arcee-py. You can manually edit it or run `inv uv`
2. Create a new release, with the name being the `__version__` of arcee-py

#### [Manual release \[not recommended\]](https://github.com/arcee-ai/arcee-python#manual-release-not-recommended) <a href="#user-content-manual-release-not-recommended" id="user-content-manual-release-not-recommended"></a>

We do not recommend this. If you need to, please make the version number an alpha or beta release.\
If you need to create a manual release, you can run `inv build && inv publish`
