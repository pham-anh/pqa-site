# Pham Quynh Anh's Site

## Build the site

Install hugo
- https://gohugo.io/getting-started/installing/

Clone this repo

```
git clone git@github.com:pham-anh/pqa-site.git
cd pqa-site
```

Download theme

```
git clone https://github.com/monkeyWzr/hugo-theme-cactus.git themes/cactus
```

Download content

```
hugo mod get -u
```

Run server

```
hugo server -D
```

Or generate static files

```
hugo -D
```

- Static files are generated in `public` directory

Upload static files to GCS

- https://gohugo.io/hosting-and-deployment/hugo-deploy/

```
gcloud auth login
export GOOGLE_APPLICATION_CREDENTIALS="path/to/serviceAccountKeyFile.json"
hugo deploy
```

From here, use Google Cloud load balancer with GCS as the backend to publish the site to the internet.
