# LeRobot: State-of-the-art AI for Real-World Robotics

LeRobot provides models, tools, and pretrained policies for robotics in PyTorch. The goal is to make robotics research accessible and reproducible.

## Quick Setup

Clone the repo and install dependencies:
```bash
git clone https://github.com/kylekam/lerobot.git #Our branch
git checkout gatech/reproduce_results
cd lerobot
conda create -y -n lerobot python=3.10
conda activate lerobot
pip install -e .
pip install 'lerobot[pusht]' hydra-core # For our task
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
python src/lerobot/scripts/lerobot_train.py \
  --policy.type=diffusion \
  --env.type=pusht \
  --dataset.repo_id=lerobot/pusht \
  --policy.push_to_hub=false \
  --dataset.image_transforms.enable=true \
  --eval_freq=10000 \
  --log_freq=200 \
  --save_freq=25000 \
  --wandb.enable=false \
  --output_dir=outputs/train/diffusion_pusht
```

Evaluate a pretrained policy:
```bash
python src/lerobot/scripts/lerobot_eval.py \
    --policy.path={model_file} \
    --env.type=pusht \
    --eval.n_episodes=10 \
    --eval.batch_size=1 \
    --policy.device=cuda \
    --output_dir=./eval_output 
```

Note: Use --eval.vis_noise=True for visualization

Checkpoints are saved in `outputs/train/<date>/<experiment>/checkpoints/`. 

To resume training:
```bash
python lerobot/scripts/train.py hydra.run.dir=<experiment_dir> resume=true
```

## Directory Structure

- `examples/` — Example scripts for training, evaluation, and usage
- `src/` — Core library, configs, and scripts
- `outputs/` — Results, logs, checkpoints
- `tests/` — Pytest utilities

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
