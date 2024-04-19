### Dependencies
```
pip install -e .
pip install -e ".[webui]"
```

# With logs access
"""
### Get logs
```
gsutil -m rsync -r gs://fastchat_logs ~/fastchat_logs/
```

### Clean battle data
```
cd ~/FastChat/fastchat/serve/monitor
python3 clean_battle_data.py
```
"""

# Without logs access
"""
### Get the notebook link from the original app.py:
```
https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard/blob/main/app.py
#Line 13
notebook_url = https://colab.research.google.com/drive/1KdwokPjirkTmpO_P1WByFNFiqxWQquwH#scrollTo=cWr1RMsqxWGg
```

### Get the google drive link for the clean_battle_DATE.json from the notebook
```
https://drive.google.com/file/d/1_72443egRzwRTmJfIyOQcf1ug7sKbqbX/view?usp=sharing
#...
cd fastchat/serve/monitor
gdown --id 1_72443egRzwRTmJfIyOQcf1ug7sKbqbX
```
"""

### Run Elo analysis
```
python3 elo_analysis.py --clean-battle-file clean_battle_20240329.json
```

### Copy files to HF space
1. Get lastest leaderboard_table
```
wget https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard/raw/main/leaderboard_table_20240329.csv
```

### Update files on webserver
```
DATE=20231002

rm -rf elo_results.pkl leaderboard_table.csv
wget https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard/resolve/main/elo_results_$DATE.pkl
wget https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard/resolve/main/leaderboard_table_$DATE.csv
ln -s leaderboard_table_$DATE.csv leaderboard_table.csv
ln -s elo_results_$DATE.pkl elo_results.pkl
```
