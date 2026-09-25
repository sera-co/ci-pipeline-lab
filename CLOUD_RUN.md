# Cloud Run Mapping

The Docker Hub deployment maps to Google Cloud Run as follows:

| Current pipeline stage | Cloud Run equivalent |
| --- | --- |
| Build and push to Docker Hub | Build the container and push it to Google Artifact Registry, for example `REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY/app:${GITHUB_SHA}`. |
| Deploy with Docker Compose | Deploy the Artifact Registry image with `gcloud run deploy APP_NAME --image REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY/app:${GITHUB_SHA} --region REGION`. |
| Docker Hub username and access token | Authenticate GitHub Actions with a Google Cloud service account, preferably using Workload Identity Federation, and grant it permission to push to Artifact Registry and deploy to Cloud Run. |

This note is documentation only; this project does not deploy to Cloud Run.