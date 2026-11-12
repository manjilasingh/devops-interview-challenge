# DevOps Hands-On Challenge

This round has **5 parts**.

- Please talk out loud as you work, so we can follow your thinking.
- You can use Google, documentation and `--help`.
- It's OK if you don't finish everything. We care more about how you work than how much you finish.

| Part | Topic | 
|------|-------|
| 1 | Docker |
| 2 | CI pipeline |
| 3 | AWS |
| 4 | Log script |
| 5 | Terraform |

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

---

## Part 4: Log script

**File:** `logs/access.log` (sample logs)

You are on call and need a quick tool to check application logs.

Each log line looks like this:

```
<timestamp> <client_ip> <method> <path> <status_code> <latency_ms>
```

**Task:** Write a script in Python or Bash (your choice). It should read log
lines from standard input, like this:

```bash
python3 your_script.py < logs/access.log
```

It should print:

1. The 5xx error rate for each endpoint (path), sorted from highest to
   lowest.
2. Every one-minute window where the 5xx error rate is above 20%.
   Only include minutes with at least 3 requests.
3. How many bad lines were skipped.

The script must not crash on bad input.

Expected output for `logs/access.log`:

```
Endpoint error rates:
/api/orders   2/5   40.0%
/api/users    0/3   0.0%

Alert windows (>20% 5xx, min 3 requests):
2026-10-04T10:15   2/4   50.0%

Skipped malformed lines: 1
```

---

## Part 5: Terraform

**File:** `terraform/main.tf`

A teammate wrote this Terraform file to create a private `team-reports` S3 bucket.

**Task 1: Make it valid**

Run these commands in the `terraform/` folder:

```bash
terraform init
terraform validate
```

It fails right now. Fix the file until `terraform validate` says:

```
Success! The configuration is valid.
```

**Task 2: Review it**

The file is now valid, but is it safe to use for real? Tell us what you
would change and why.
