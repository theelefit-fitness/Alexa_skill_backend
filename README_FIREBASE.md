# Firebase Setup Instructions

Your Firebase service account key has expired, causing the `"invalid_grant: account not found"` error. Here's how to create a new one:

## Step 1: Generate a New Service Account Key

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Select your project: `theelefit-3f6c6`
3. Click the ⚙️ (gear icon) next to "Project Overview" and select "Project settings"
4. Go to the "Service accounts" tab
5. Click "Generate new private key" button at the bottom of the Firebase Admin SDK section
6. Click "Generate key" to download a new JSON file

## Step 2: Replace the Service Account Key

1. Copy the contents of the downloaded JSON file
2. Replace the contents of `/home/vanamabhinav/fitness /Fitness_Tracker/backend/serviceAccountKey.json` with the new key
3. Restart your backend server

## Step 3: Test Firebase Connection

Run the backend with TEST_MODE set to False and send a test request:

```bash
cd ~/fitness\ /Fitness_Tracker/backend
source venv/bin/activate
python app.py
```

In another terminal, send a test request:

```bash
curl -X POST http://127.0.0.1:5000/api/log-workout \
  -H "Content-Type: application/json" \
  -d '{"workoutType":"running","activityName":"jogging","duration":30,"timestamp":"2023-08-11","source":"test"}'
```

You should get a response with `"success": true` and a real Firebase ID in the `workout_id` field.

## Verifying Data in Firebase

To verify the data was stored:

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Select your project: `theelefit-3f6c6`
3. Click "Realtime Database" in the left sidebar
4. You should see your data under the "workout_logs" or "meal_logs" collections

## Note on Service Account Keys

Service account keys have permission to access your Firebase project. Keep them secure and don't commit them to public repositories. 