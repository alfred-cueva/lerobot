# LeRobot: State-of-the-art AI for Real-World Robotics

LeRobot provides models, tools, and pretrained policies for robotics in PyTorch. The goal is to make robotics research accessible and reproducible.

## Quick Setup

Clone the repo and install dependencies:
```bash
git clone https://github.com/huggingface/lerobot.git
cd lerobot
git checkout add_transformer_diffusion_model  # Switch to the correct branch
conda create -y -n lerobot python=3.10
conda activate lerobot
pip install -e .
```

> **Note:** If you encounter build errors, install `cmake` and `build-essential`:
> ```bash
> sudo apt-get install cmake build-essential
> ```

## Experiment Tracking

To use [Weights and Biases](https://docs.wandb.ai/quickstart) for logging:
```bash
wandb login
```
Enable WandB in your config with `wandb.enable=true` when running training/evaluation scripts.

![wandb log example](media/wandb.png)

## Training and Evaluation

Train a policy:
```bash
python lerobot/scripts/train.py policy=diffusion env=pusht wandb.enable=true
```

Evaluate a pretrained policy:
```bash
python lerobot/scripts/eval.py -p lerobot/diffusion_pusht eval.n_episodes=10 eval.batch_size=10
```

Checkpoints are saved in `outputs/train/<date>/<experiment>/checkpoints/`. Each checkpoint contains:
- `pretrained_model/` with `model.safetensors`, `config.json`, `config.yaml`
- `training_state.pth`

To resume training:
```bash
python lerobot/scripts/train.py hydra.run.dir=<experiment_dir> resume=true
```

## Directory Structure

- `examples/` — Example scripts for training, evaluation, and usage
- `lerobot/` — Core library, configs, and scripts
- `outputs/` — Results, logs, checkpoints
- `tests/` — Pytest utilities

## Contributing

See [CONTRIBUTING.md](https://github.com/huggingface/lerobot/blob/main/CONTRIBUTING.md) for guidelines.

## Citation

If you use LeRobot, please cite:
```bibtex
@misc{cadene2024lerobot,
    author = {Cadene, Remi et al.},
    title = {LeRobot: State-of-the-art Machine Learning for Real-World Robotics in Pytorch},
    howpublished = "\url{https://github.com/huggingface/lerobot}",
    year = {2024}
}
```

For pretrained models or policies, cite the original works as appropriate.
