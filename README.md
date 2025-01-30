# ollamaCPUoptimizer
optiize settings for ollama as a single file

check cpu cores
```bash
lscpu | grep "^CPU(s):"
```
Memory-Based Cache (memory): Faster but consumes more RAM<br />
File-Based Cache (file): Slower but conserves RAM by using disk storage
```bash```
echo 'export OLLAMA_KV_CACHE_TYPE=file' >> ~/.bashrc
```
```bash
source ~./bashrc
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

# diagnostics
```bash
sudo apt install htop free
```Set Up Automated Alerts (Advanced)
For proactive management, set up alerts to notify you when memory usage exceeds certain thresholds.

Using cron and mail:

Install mailutils:

BASH

sudo apt install mailutils -y
Create a Monitoring Script:

BASH

nano ~/monitor_ollama.sh
Add the Following Content:

BASH

#!/bin/bash

# Threshold in MB
THRESHOLD=4000

# Get memory usage of ollama in MB
USED=$(ps -o rss= -C ollama | awk '{sum += $1} END {print sum/1024}')

# Compare and send email if exceeded
EXCEEDED=$(echo "$USED > $THRESHOLD" | bc)
if [ "$EXCEEDED" -eq 1 ]; then
    echo "Ollama is using ${USED}MB of RAM which exceeds the threshold of ${THRESHOLD}MB." | mail -s "Ollama Memory Alert" your_email@example.com
fi
Make the Script Executable:

BASH

chmod +x ~/monitor_ollama.sh
Set Up a Cron Job:

BASH

crontab -e
Add the Following Line to Run Every 5 Minutes:

BASH

*/5 * * * * /home/your_username/monitor_ollama.sh
Replace your_username and your_email@example.com accordingly.
