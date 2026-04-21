# FastAPI Iris Classifier

FastAPI app for the TDS iris classifier assignment.

Run locally:

```powershell
pip install -r requirements.txt
uvicorn app:app --host 0.0.0.0 --port 8000
```

Test:

```powershell
curl "http://localhost:8000/health"
curl "http://localhost:8000/predict?sl=6.6&sw=4.3&pl=1.9&pw=1.9"
```
