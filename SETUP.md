# Setup

## Requirements

- A Snapdragon-powered Windows PC (Snapdragon X series). If you do not have one, model profiling can be done on Qualcomm AI Hub's hosted devices, but the live app cannot be run.
- Windows 11.
- **Python:** Qualcomm's `qai_hub_models` tooling on Windows on ARM has required an **x64** Python install rather than ARM64. Check the current Qualcomm AI Hub documentation before installing.
- A free Qualcomm AI Hub account and API token.
- A working microphone (for recording mode).

## Steps

1. Clone this repository.
2. Create and activate a virtual environment.
3. Install dependencies (see `requirements.txt` once added).
4. Configure your AI Hub API token as described in the Qualcomm AI Hub documentation.
5. Download the speech and language models (one-time, needs internet).
6. Disconnect from the network and run the app to confirm it works offline.

Record the exact commands you used and the versions of Python, ONNX Runtime and the AI Hub packages here.

## Troubleshooting

Add problems you hit and their fixes here as you go. Environment setup on Windows on ARM is the most likely place to lose time.
