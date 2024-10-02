# OmniBench

The project introduces **OmniBench**, a novel benchmark designed to rigorously evaluate models' ability to recognize, interpret, and reason across **visual**, **acoustic**, and **textual** inputs simultaneously. We define models capable of such tri-modal processing as omni-language models (OLMs).

Results could also be found at the [live leaderboard]([https://m-a-p.ai/OmniBench/#leaderboard](https://ertyuiocvbnm.github.io/OmniBench#leaderboard)).

## Inference

### Evaluation Example with OpenAI Style API Call

```shell
python inference/demo_api_call.py --output-file your_model_inference_output.json
```

Run the ablation setting without image (audio+text) or without audio (image+text).
```shell
python inference/demo_api_call.py --no-image --output-file your_model_inference_output.no-image.json
python inference/demo_api_call.py --no-audio --output-file your_model_inference_output.no-image.json
```

### Parsing and Evaluation

```shell
python inference/calculate_metrics.py --input-file dataset/batch-5_1142_20240817.jsonl --inference-file your_model_inference_output.jsonl
```

## Dataset

The dataset consists of the following keys:
- `"index"`: an integer suggests the question id.
- `"task type"`: a string suggests one of the 7 task types.
- `"audio type"`: a string suggests one of the 3 audio types (speech, sound event and music).
- `"question"`: a string suggests the question.
- `"options"`: a list of four strings for multi-choice questions.
- `"answer"`: a string suggesting the correct response, must appear in `"options"`.
- `"audio_path"`: the basename of the audio file, need to prepend `mm_data/audio` before using.
- `"image_path"`: the basename of the image file, need to prepend `mm_data/image` before using.
- `"audio"` (for HF version only): contains the numpy array for the wavfile.
- `"image"` (for HF version only): contains the `PIL.Image()` object for the image.
- `"audio content"`: the human-annotated audio transcripts, used in text alternative experiments.
- `"image content"`: the VLM-generated caption for the image, used in text alternative experiments.

### Download from Github

The local version data is placed at `dataset/batch-5_1142_20240817.jsonl`. You will need to use `git lfs` to pull the folder `mm_data` for the images and audios.
