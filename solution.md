# Question 3: Deploy a FastAPI Iris Classifier

## Final submission

Pending deployment URL.

Local verification passed:

```json
{"prediction": 0, "class_name": "setosa"}
```

Public repo:

```text
https://github.com/sriv144/tds-fastapi-iris-q3
```

Render Blueprint deploy link:

```text
https://dashboard.render.com/blueprint/new?repo=https://github.com/sriv144/tds-fastapi-iris-q3
```

## ELI15 step-by-step solution

1. Make a FastAPI app.

   FastAPI is a Python tool for making web APIs. An API endpoint is just a URL that returns data, usually JSON.

2. Load the iris dataset.

   The iris dataset has flower measurements and labels. The labels are:

   - `0` = `setosa`
   - `1` = `versicolor`
   - `2` = `virginica`

3. Train a Decision Tree model.

   The app loads the iris data when it starts, creates a `DecisionTreeClassifier(random_state=42)`, and trains it using:

   ```python
   model.fit(iris.data, iris.target)
   ```

4. Add a health endpoint.

   `GET /health` returns:

   ```json
   {"status": "ok"}
   ```

   This is a quick way to check whether the app is alive.

5. Add a prediction endpoint.

   `GET /predict?sl=X&sw=X&pl=X&pw=X` accepts four flower measurements:

   - `sl` = sepal length
   - `sw` = sepal width
   - `pl` = petal length
   - `pw` = petal width

   It returns JSON like:

   ```json
   {"prediction": 0, "class_name": "setosa"}
   ```

6. Test the unique sample.

   The assignment sample is:

   ```text
   sl=6.6, sw=4.3, pl=1.9, pw=1.9
   ```

   Request:

   ```text
   /predict?sl=6.6&sw=4.3&pl=1.9&pw=1.9
   ```

   Expected result:

   ```json
   {"prediction": 0, "class_name": "setosa"}
   ```

7. Deploy the app.

   The project supports Vercel, which gives an accepted `*.vercel.app` URL. The root `app.py` contains the FastAPI app, and `api/index.py` imports it so Vercel can serve it as a Python serverless function.

   I also added `render.yaml`, so it can be deployed on Render as a web service using:

   ```text
   https://dashboard.render.com/blueprint/new?repo=https://github.com/sriv144/tds-fastapi-iris-q3
   ```

8. Submit only the deployed app URL.

   The grader will call `/health` and `/predict` on that deployed URL.

## Files used

- `app.py`: FastAPI application and model
- `api/index.py`: Vercel entry point
- `requirements.txt`: Python dependencies
- `vercel.json`: Vercel routing

## Ask AI notes

- A FastAPI app can be deployed on free platforms such as Hugging Face Spaces, Vercel, or Render. For this assignment, the grader accepts only `*.hf.space`, `*.vercel.app`, or `*.onrender.com`.
- `uvicorn` is the ASGI server that runs FastAPI directly. `gunicorn` is a process manager often used in production on Linux, commonly with Uvicorn workers. For a small assignment API, `uvicorn` locally and Vercel's Python runtime in deployment are enough.
- FastAPI validates query parameters automatically from type hints like `sl: float`. If a required query parameter is missing or not a number, FastAPI returns a `422 Unprocessable Entity` response. A working request returns `200 OK`.
