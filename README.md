GoHugo based static site for Springbok LLC

#IMPORTANT:
Website runs on hugo v76.5 (https://github.com/gohugoio/hugo/releases/tag/v0.76.5). Later versions of hugo will break the site. Download and rename as seperate bin ~ eg, bin/hugo76.5. See https://github.com/okkur/syna/issues/851 for details

## Deploy:
Use `hugo76.5` to move current changes into public folder
`hugo76.5` does not delete generated files, so deleting public/ before running `hugo` is good practice
`hugo76.5 deploy --target=s3` to deploy public/ to s3. Location of deployment can be modified in config.toml
`hugo76.5 deploy --target=www` to deploy to second bucket
`hugo76.5 deploy --target=staging` to deploy to staging bucket

staging site url: http://springbok-hugo-site.s3-website-us-east-1.amazonaws.com/
