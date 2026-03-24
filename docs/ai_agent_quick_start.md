# AI Agent Quick Start

This guide is for the most common user workflow in this repository:

1. you describe an object or asset idea in plain language;
2. an AI coding agent writes the blueprint file;
3. you build the result through the GUI or CLI;
4. you inspect it and iterate.

You do not need to write blueprint code by hand to use PixelVox Factory.

## What To Give The Agent

Tell the agent to read these repository files before writing the blueprint:

- [README.md](README.md)
- [docs/architecture_overview.md](docs/architecture_overview.md)
- [templates/vox_blueprint_template.py](templates/vox_blueprint_template.py) for voxel assets
- [templates/pixel_blueprint_template.py](templates/pixel_blueprint_template.py) for pixel-art assets
- one or two relevant examples from `vox_blueprints/` or `pixel_blueprints/`

Tell the agent where to save the file:

- voxel blueprints go in `vox_blueprints/`
- pixel-art blueprints go in `pixel_blueprints/`

## What The Agent Should Produce

For voxel output, the agent should create a Python file that exposes:

```python
def make_model(x, y, z, W, D, H):
    ...
    return color_index_or_zero
```

For pixel-art output, the agent should create a Python file that exposes:

```python
def make_image(x, y, W, H):
    ...
    return color_index_or_zero
```

The file should also follow the existing repository style:

- readable geometry-first logic;
- sensible default dimensions;
- short display name and description;
- optional palette overrides only when they help the asset read correctly.

## Ready-To-Paste Prompt For A Voxel Asset

```text
Create a new voxel blueprint for this repository.

Before writing code, read README.md, docs/architecture_overview.md, and templates/vox_blueprint_template.py. Also inspect one or two existing examples in vox_blueprints/ to match the repository style.

I want: a small stylized car.

Requirements:
- save the file under vox_blueprints/
- follow the existing make_model(x, y, z, W, D, H) contract
- keep the code readable and compact
- add sensible DEFAULT_W, DEFAULT_D, DEFAULT_H values
- add BLUEPRINT_DISPLAY_NAME and BLUEPRINT_DESCRIPTION
- use the public vox_art.engine facade only
- make it buildable through python -m vox_art.build_blueprint

After writing the file, briefly explain which dimensions and shape decisions you chose.
```

## Ready-To-Paste Prompt For A Pixel-Art Asset

```text
Create a new pixel-art blueprint for this repository.

Before writing code, read README.md, docs/architecture_overview.md, and templates/pixel_blueprint_template.py. Also inspect one or two existing examples in pixel_blueprints/ to match the repository style.

I want: a tiny top-down car icon.

Requirements:
- save the file under pixel_blueprints/
- follow the existing make_image(x, y, W, H) contract
- keep the code readable and compact
- add sensible DEFAULT_W and DEFAULT_H values
- add BLUEPRINT_DISPLAY_NAME and BLUEPRINT_DESCRIPTION
- use the public pixel_art.engine facade only
- make it buildable through python -m pixel_art.build_blueprint

After writing the file, briefly explain which palette and silhouette decisions you chose.
```

## After The Agent Writes The File

You do not need to understand every line of the blueprint before trying it.

The normal next step is simply to build it.

For voxel output:

```bash
python -m vox_art.build_blueprint your_blueprint_name
```

For pixel-art output:

```bash
python -m pixel_art.build_blueprint your_blueprint_name
```

Or launch the GUI and select the new blueprint there.

## When To Use Manual Authoring Docs Instead

Use [docs/first_blueprint.md](docs/first_blueprint.md) only if you want to write or edit blueprint code by hand.

That document is for manual authoring, not for the normal AI-assisted beginner workflow.