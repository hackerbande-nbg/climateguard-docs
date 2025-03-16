# Service Setup

| Service Name | Port | Description | URL |
| ------------ | ---- | ----------- | --- |
| quantum stage web |8001| quantum stage web server hosted in docker | https://api-stage.quantum.hackerban.de/ |
| quantum stage db |8003| quantum stage postgres db hosted in docker |
| quantum prod web |8000| quantum prod web server hosted in docker | https://api.quantum.hackerban.de/ |
| quantum prod db |8000| quantum prod postgres db hosted in docker |
| nginx reverse proxy |80:81:443| nginx reverse proxy in docker | http://quantum.hackerban.de:81 |
