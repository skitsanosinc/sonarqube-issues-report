# skitsanosinc/sonarqube-issues-report
>  A GitHub Action for generating SonarQube Code Issues Report

This action will reach out to your SonarQube API URL, extract unresolved issues, collecting only the following fields:

- key
- component
- project
- textRange
- severity

Extracted data will be uploaded to our API and unique `RUN_ID` will be generated all together with `PREVIEW_URL` - URL where code issues can be seen.



## How to use

Example of how to use this action:

```yaml
name: SonarQube Report

on:
  workflow_dispatch:

jobs:
  scan:
    name: Generate Report
    runs-on: ubuntu-latest
    steps:
      - uses: skitsanosinc/sonarqube-qualitygate-generate-report@main
        id: report-generator
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
          SONAR_HOST_URL: ${{ secrets.SONAR_HOST_URL }}
          SONAR_PROJECT: default-dashboard

      - run: |
          echo "output: ${{ steps.report-generator.outputs.PREVIEW_URL }}"
```