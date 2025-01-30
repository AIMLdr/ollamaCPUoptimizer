# ollamaCPUoptimizer
optiize settings for ollama as a single file

check cpu cores
```bash
lscpu | grep "^CPU(s):"
```


```bash
nano ~/.bashrc
```
```text
# Ollama CPU Optimization
export OLLAMA_NUM_PARALLEL=8                       # Adjust based on your CPU's thread count
export OLLAMA_KV_CACHE_TYPE=memory                 # Options: 'file' or 'memory'
export OLLAMA_KEEP_ALIVE=10m                       # Connection keep-alive duration
export OLLAMA_HOST=http://127.0.0.1:11434          # Server host and port
export OLLAMA_MODELS=/home/hacker/.ollama/models   # Path to your models
export OLLAMA_MAX_QUEUE=256                        # Maximum number of queued requests
export OLLAMA_NOHISTORY=false                      # Enable or disable history
export GIN_MODE=release                            # Run in release mode for better performance
```
```bash
source ~/.bashrc
```
