### LLM Learning

#### Build vLLM from here: https://github.com/ssakar/tutorial/tree/main/vllm

```bash 
 podman run --rm --device nvidia.com/gpu=all --security-opt=label=disable \
  --net=host --ipc=host \
  -v ~/.cache:/root/.cache \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "VLLM_ATTENTION_BACKEND=FLASHINFER" \
  vllm-cu128 vllm serve solidrust/Mistral-7B-Instruct-v0.3-AWQ \
    --quantization awq_marlin \
    --dtype float16 \
    --gpu-memory-utilization 0.90 \
    --max-model-len 2048 \
    --enable-prefix-caching \
    --enable-auto-tool-choice \
    --tool-call-parser mistral \
    --chat-template examples/tool_chat_template_mistral_parallel.jinja

```

```bash
podman run --rm --device nvidia.com/gpu=all --security-opt=label=disable \
  --net=host --ipc=host \
  -v ~/.cache:/root/.cache \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "VLLM_ATTENTION_BACKEND=FLASHINFER" \
  vllm-cu128 vllm serve hugging-quants/Meta-Llama-3.1-8B-Instruct-AWQ-INT4 \
    --quantization awq_marlin \
    --dtype float16 \
    --gpu-memory-utilization 0.90 \
    --max-model-len 2048 \
    --enable-prefix-caching \
    --enable-auto-tool-choice \
    --tool-call-parser llama3_json \
    --chat-template examples/tool_chat_template_llama3.1_json.jinja
```