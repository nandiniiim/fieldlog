# FieldLog

**Offline interview-to-record assistant for Snapdragon-powered HP PCs.**

Submission for the Snapdragon® AI Lab Build & Present Challenge.

FieldLog turns a recorded field interview into a structured, exportable record entirely on the laptop, with no internet connection. Speech recognition and a small language model run on the Snapdragon NPU, so nothing is ever sent to the cloud.

> **Status: in development.** See [Project status](#project-status) for exactly what works today. Nothing in this repository claims results that have not been measured.

---

## The problem

Field researchers, surveyors, NGO workers and students often interview people where connectivity is poor or absent. Cloud transcription and cloud AI assistants do not work there. Interviews also contain personal information (names, locations, livelihoods, opinions), and sending raw audio to third-party servers is a consent and data-protection risk. The usual result is handwritten notes, then hours of retyping and structuring afterwards, with details lost along the way.

## What FieldLog does

1. **Record** an interview, or load an existing audio file.
2. **Transcribe** locally with a speech-recognition model on the NPU.
3. **Structure** the transcript locally with a quantized small language model into a fixed schema (see [`schema/interview_schema.json`](schema/interview_schema.json)): respondent details, key issues, notable quotes, follow-ups.
4. **Review and edit** the extracted fields, so the user stays in control.
5. **Export** to CSV or JSON, one row per interview.

The application is designed to work with the network disabled.

## Why on-device, and why the NPU

- Offline use makes local inference the only option, not a preference.
- Continuous transcription plus LLM inference is a sustained AI workload. The NPU is what makes that practical on battery in the field.
- Keeping audio on the device is a privacy property that can be demonstrated directly: turn the network off and the tool still works.

## Models and runtime

| Stage | Model source | Runtime |
|---|---|---|
| Speech-to-text | Whisper (English), Qualcomm AI Hub | ONNX Runtime with QNN execution provider, Hexagon NPU |
| Structuring | Quantized Llama 3.2 3B or Phi-3.5 mini, Qualcomm AI Hub | On-device LLM deployment via AI Hub tooling |
| App layer | none | Python with a lightweight UI |

No model is trained or fine-tuned. All models are pre-trained and used under their own licenses. The exact model chosen for each stage will be recorded in [`docs/PROFILING.md`](docs/PROFILING.md) once tested on hardware.

## Architecture

See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the pipeline diagram and design decisions.

## Getting started

See [`docs/SETUP.md`](docs/SETUP.md).

## Project status

- [ ] Environment set up on Snapdragon hardware
- [ ] One AI Hub model running on the NPU
- [ ] End-to-end transcription of an audio file
- [ ] LLM structuring into the fixed schema
- [ ] Review screen and CSV/JSON export
- [ ] NPU vs CPU profiling results published
- [ ] Demo video (recorded in airplane mode)

Tick these off only as they are actually done.

## Scope and known limitations

- **English audio only** in the first version. Local-language and code-mixed interviews are out of scope.
- **Small models make mistakes.** The LLM can miss details or produce invalid output. The app validates output against the schema, retries once, then falls back to the raw transcript for manual entry. Every field is editable before export.
- Out of scope: model training, cloud sync, user accounts, speaker separation, mobile apps.

## Ethics and data handling

- Audio and transcripts stay on the local machine.
- Test recordings must use consenting volunteers or scripted material. Do not commit real respondent data to this repository.
- The `.gitignore` excludes audio files and outputs by default.

## License

MIT. See [`LICENSE`](LICENSE). Third-party models remain under their own licenses.

## Author

Nandini, India.
