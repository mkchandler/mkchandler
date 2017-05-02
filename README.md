# mkchandler.com

My official web site containing my blog, with more content coming soon.

## Requirements

I've tested building and running this site with the following:

- [Ruby v2.3.0+](https://www.ruby-lang.org)

## Usage

To build the site locally:

    $ bundle install
    $ bundle exec jekyll build

If you would like to start the local development server, which will also watch
for changes:

    $ bundle exec jekyll serve

Build and run in production mode (bundles/minifies assets):

    $ JEKYLL_ENV=production bundle exec jekyll serve

## Deployment

The site is hosted on [AWS](https://aws.amazon.com) using the following stack:

- [S3](https://aws.amazon.com/s3/): Bucket for all of the static assets
- [CloudFront](https://aws.amazon.com/cloudfront/): Content delivery and caching
- [Route 53](https://aws.amazon.com/route53/): DNS for mkchandler.com
- [Certificate Manager](https://aws.amazon.com/certificate-manager/): TLS certificate for mkchandler.com

Builds and deployments happen automatically when changes are pushed to master
using:

- [CodePipeline](https://aws.amazon.com/codepipeline/): Watches for changes on the GitHub repo
- [CodeBuild](https://aws.amazon.com/codebuild/): Builds the site in production mode and drops assets in S3
