# Terrains for Quadrupeds

Repo for setting up **custom terrains** to train and test quadruped robots (Go2, ANYmal, Spot, etc.) in **Isaac Sim / IsaacLab**.

The goal is to make it easy to:

- Download or generate realistic outdoor terrains.
- Convert them into **USD** / heightfields compatible with Isaac Sim / IsaacLab.
- Plug them into standard locomotion tasks (e.g., `Locomotion > Velocity > Rough`).

---

## Features

- **Programmatic terrains in IsaacLab**
  - Wavy / slope / step / random block terrains as heightfields or meshes.
- **Infinigen → Blender → Isaac Sim pipeline**
  - Generate photorealistic outdoor scenes in Infinigen.
  - Export to USD/OBJ and bring them into Isaac Sim as environments.
- **Online asset → Isaac Sim pipeline**
  - Take CC0 terrains (OBJ/FBX, etc.) and convert them to Sim-ready USD.
- **Example quadruped tasks**
  - Simple IsaacLab example config to run a quadruped on these terrains.

---

## Repo structure

```text
isaaclab_terrains/       # programmatic terrains, configs, scripts
pipelines/               # step-by-step guides (Infinigen, web assets)
assets/                  # example heightfields and USD terrains
examples/                # IsaacLab / Isaac Sim examples
media/                   # screenshots and gifs for documentation
```

## Requirements
This repo assumes you already have:

- NVIDIA Isaac Sim (version 4.5)
- IsaacLab 2.0
- Python ≥ 3.10
- numpy, matplotlib (for terrain generation / visualization)

You’ll typically launch scripts using Isaac Sim’s Python:
```bash
./python.sh path/to/script.py
```

## 1. Preview a programmatic terrain in Isaac Sim
Clone the repo:
```bash
git clone https://github.com/rushabhdhoke/Terrains_for_Quadrupeds.git
cd Terrains_for_Quadrupeds
```

Generate a simple wavy heightfield:
```bash
./python.sh isaaclab_terrains/scripts/generate_wavy_heightfield.py
```
- This script writes a small heightmap (e.g. assets/heightfields/wavy_terrain.npy).
- In Isaac Sim / IsaacLab, load a simple environment that uses this heightfield
(example config in examples/isaaclab_go2_rough_terrain/go2_rough_terrain_env_cfg.py).
- Spawn your quadruped and run the base locomotion task.

## 2. Infinigen → Blender → Isaac Sim
- High-level pipeline (documented in pipelines/infinigen_to_isaac/README.md):
- Use Infinigen to generate a terrain (forest, rocky field, etc.).
- Export the scene or terrain mesh to USD / OBJ using Infinigen’s export utilities.
- Open the exported asset in Blender to fix scale, pivot, and materials.
- Export from Blender to USD with Omniverse-friendly settings.
Import the USD into Isaac Sim as an environment and plug it into your quadruped task.

3. Online asset → Isaac Sim
- High-level pipeline (documented in pipelines/web_assets_to_isaac/README.md):
- Download a CC0 terrain (OBJ/FBX, etc.).
- Clean and rescale in Blender (units = meters).
- Export as USD.
- Import into Isaac Sim and save to your assets/usd/ folder.
