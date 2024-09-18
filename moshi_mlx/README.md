# Moshi - MLX

See the [top-level README.md][main_repo] for more information on Moshi.

[Moshi][moshi] is a speech-text foundation model and full-duplex spoken dialogue framework.
It uses [Mimi][moshi], a state-of-the-art streaming neural audio codec. Mimi operates at a framerate of 12.5 Hz, and compress
24 kHz audio down to 1.1 kbps, in a fully streaming manner (latency of 80ms, the frame size), yet performs better than existing, non-streaming, codec.

This is the MLX implementation for Moshi. For Mimi, this uses our Rust based implementation through the Python binding provided in `rustymimi`, available in the [rust/](https://github.com/kyutai-labs/moshi/tree/main/rust) folder of our main repository.

## Requirements

You will need at least Python 3.10.

```bash
pip install moshi_mlx  # moshi MLX, from PyPI
# Or the bleeding edge versions for Moshi and Moshi-MLX.
pip install -e "git+https://git@github.com/kyutai-labs/moshi#egg=moshi_mlx&subdirectory=moshi_mlx"
```
We have tested the MLX version with MacBook Pro M3.

If you get an error when installing `moshi_mlx` or `rustymimi` (which `moshi_mlx` depends on),
you might need to install the [Rust toolchain](https://rustup.rs/) to install `rustymimi` from sources.


## Usage


Once you have installed `moshi_mlx`, you can run
```bash
python -m moshi_mlx.local -q 4   # weights quantized to 4 bits
python -m moshi_mlx.local -q 8   # weights quantized to 8 bits
# And using a different pretrained model:
python -m moshi_mlx.local -q 4 --hf-repo kmhf/moshika-mlx-q4
python -m moshi_mlx.local -q 8 --hf-repo kmhf/moshika-mlx-q8
# be careful to always match the `-q` and `--hf-repo` flag.
```

This uses a command line interface, which is barebone. It does not perform any echo cancellation,
nor does it try to compensate for a growing lag by skipping frames.

You can use `--hf-repo` to select a different pretrained model, by setting the proper Hugging Face repository.
See [the model list](https://github.com/kyutai-labs/moshi?tab=readme-ov-file#models) for a reference of the available models.

Alternatively you can use `python -m moshi_mlx.local_web` to use
the web UI, the connection is via http, at [localhost:8998](http://localhost:8998).


## License

The present code is provided under the MIT license.

## Citation

If you use either Mimi or Moshi, please cite the following paper,

```
@article{defossez2024moshi,
    title={Moshi: a speech-text foundation model for real-time dialogue},
    author={Alexandre Défossez and Laurent Mazaré and Manu Orsini and Amélie Royer and
            Patrick Pérez and Hervé Jégou and Edouard Grave and Neil Zeghidour},
    journal={arXiv:TBC},
    year={2024},
}
```

[moshi]: https://kyutai.org/Moshi.pdf
[main_repo]: https://github.com/kyutai-labs/moshi