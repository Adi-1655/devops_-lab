# devops_-lab

## Jenkins: build and deploy on every push

This repository is a static website. Its `Jenkinsfile` checks out the configured GitHub source, validates `index.html`, and copies the site files to `C:\inetpub\wwwroot` on a Windows Jenkins agent.

### Jenkins setup

1. Install the **Pipeline**, **Git**, and **GitHub** plugins in Jenkins. Install Git and [HTML Tidy](https://www.html-tidy.org/) on the Windows agent and ensure they are available on its `PATH`.
2. Create a Jenkins **Pipeline** job. Under **Pipeline**, select **Pipeline script from SCM**, choose **Git**, enter this repository's clone URL and credentials if needed, and set the script path to `Jenkinsfile`.
3. Ensure the job runs on a Windows agent with permission to write to `C:\inetpub\wwwroot`. The target folder should be served by IIS if you want to view the deployed site at `http://localhost/`.
4. Configure a webhook in the GitHub repository under **Settings → Webhooks → Add webhook**:
   - **Payload URL:** `https://<your-public-jenkins-url>/github-webhook/`
   - **Content type:** `application/json`
   - Select **Just the push event**.
   - Jenkins must be reachable from GitHub over HTTPS (or through a properly secured, reachable endpoint).
5. Save the job and webhook, then push a commit. Jenkins should start a run; check the job's build history and console output if it does not.

The `githubPush()` trigger in the Jenkinsfile enables webhook-triggered runs when the GitHub plugin is installed. GitHub cannot deliver webhooks to a Jenkins server that is only reachable on a private/local network; expose it securely or use a secured webhook relay/tunnel.
