# Guideline Customization

Besides some basic plugin and settings customization, we are overwriting
some ruby files in the ldap auth plugin to better integrate with ldap groups.
For future work we can pull down the plugin and it's modified gem from github.

Our configuration is `containers/web_only.yml`
We build the image as per the launcher, then we rebuild the docker image
and overwrite the two files in `file-overrides/`. All changes from the following
branches should be included in `file-overrides/` and processed correctly inside
`file-overrides/Dockerfile`.

 * https://github.com/guideline-tech/omniauth-ldap/compare/master...guideline-tech:guideline-custom?expand=1
 * https://github.com/guideline-tech/discourse-ldap-auth/compare/master...guideline-tech:guideline-custom?expand=1

## Build steps

Run docker containers for redis/postgres that discourse

 * docker run --name postgres -e POSTGRES_PASSWORD=fakestuff -e POSTGRES_USER=discourse -e POSTGRES_DB=discourse  postgres:9.5.17
 * docker run --name redis redis

Once redis and postgres are running, go ahead with these steps

 * ./launcher bootstrap web_only
 * cd file-overrides
 * docker build -t local_discourse/modified .
 * cd ../
 * docker tag local_discourse/modified us.gcr.io/staging-gl/first-pass-discourse:2
 * gcloud docker -- push us.gcr.io/staging-gl/first-pass-discourse:2

The same image appears to run fine in both staging and production
