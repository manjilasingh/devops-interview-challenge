# DevOps Hands-On Challenge

This round has **3 parts**.

- Please talk out loud as you work, so we can follow your thinking.
- You can use Google, documentation and `--help`.
- It's OK if you don't finish everything. We care more about how you work than how much you finish.

| Part | Topic | 
|------|-------|
| 1 | Docker |
| 2 | CI pipeline |
| 3 | AWS | 

---

## Part 1: Docker

**Files:** `docker/` (a small Python web app and a Dockerfile)

**Task 1: Make it work**

Build the image and run the container. When it works, this command:

```bash
curl localhost:8000
```

should return:

```json
{"message": "Hello from the container!"}
```

Right now it does not work. Find out why and fix it.

---

## Part 2: CI pipeline

**File:** `ci/build.yml`

A teammate wrote this GitHub Actions workflow. It should build the Docker
image from Part 1 and push it to Docker Hub when code is merged to `main`.

(It's in the `ci/` folder so it doesn't actually run. Normally it would be
in `.github/workflows/`.)

**Task 1:** Would you approve it? Tell us what problems you see, starting
with the most serious.

**Task 2:** Fix the problems you think matter most. You don't need to run it.

---

## Part 3: AWS 

**File:** `aws/bucket-policy.json`


A teammate wrote this policy for an S3 bucket called `team-reports`.

Only **one app** should use this bucket. The app runs as this IAM role:

```
arn:aws:iam::123456789012:role/reports-reader
```

The app only needs to **list** and **read** files. It should not be able
to do anything else.

**Task 1:** What's wrong with the current policy?

**Task 2:** Edit `aws/bucket-policy.json` so the app gets exactly what it
needs, and nothing more.
