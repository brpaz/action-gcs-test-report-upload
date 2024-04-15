#  GCS Test report upload

> A composite Github Action to upload HTML Test reports to a Google cloud storage bucket.

## ℹ️ Pre-requisites

- A Google Cloud storage (GCS) bucket configured to host websites. See [Host a static website  |  Cloud Storage  |  Google Cloud](https://cloud.google.com/storage/docs/hosting-static-website)
- A service account configured to access the specified bucket. See [How to grant access to only specific Google Cloud storage buckets using IAM conditions.](https://www.cubebackup.com/docs/ms365/tutorials365/grant-access-to-only-specific-google-cloud-storage-buckets-using-iam-conditions/)

## 🚀 Getting started

Add the following action to your workflow, after your test reports html was generated:

```yaml
- name: Upload test report
  uses: brpaz/actions-gcs-test-report-upload@main
  with:
    gcp_project_id: ${{ secrets.GCP_PROJECT_ID }}
    gcp_credentials: ${{ secrets.GCP_CREDENTIALS }}
    report_folder: "<path_to_your_report>"
    pull_request_check: "true"
    generate_summary: "true"
    github-token: ${{ secrets.GITHUB_TOKEN }}
```

You will need to configure two secrets on your repostiory:

**GCP_PROJECT_ID** - This is your project id in GCP, where your bucket lives
**GCP_CREDENTIALS** - A service account credentials key file, for your user, with access to the bucket.

### What is the URL of the report

This action will generate a [summary](https://github.blog/2022-05-09-supercharging-github-actions-with-job-summaries/) as well a Pull request check, with the URL to access report.

Note the path inside the bucket will be:

```
my-bucket/<github_repository>/<github_action_run_id>/<report-folder>
```

> [!TIP]
> If you have multiple reports generated in the same workflow, make sure to give an appropriate name to the folder, before calling this action.

## 📃 License

Distributed under the MIT License. See [LICENSE](LICENSE.md) file for details.

## 📩 Contact

- ✉️ [Email](oss@brunopaz.dev)

- 🔗 [Project Page](https://github.com/brpaz/actions-gcs-test-report-upload)
