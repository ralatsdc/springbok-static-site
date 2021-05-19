GoHugo based static site for Springbok LLC

## Deploy:
Use `hugo` to move current changes into public folder
`hugo` does not delete generated files, so deleting public/ before running `hugo` is good practice
`hugo deploy` to deploy public/ to s3. Location of deployment can be modified in config.toml