# Blackbit External Sitemaps Bundle

This Pimcore plugin allows you to include external sitemaps into your sitemap.xml. 
It also supports including external sitemap index URLs whose referenced sitemap files get resolved.

## Installation
### Composer
To get the plugin code please write an email to [info@blackbit.de](mailto:info@blackbit.de).

You then either get access to the bundle's [Bitbucket repository](https://bitbucket.org/blackbitwerbung/pimcore-plugins-external-sitemaps) or you get the plugin code as a zip file. Accessing the Bitbucket repository has the advantage that you will always see changes to the plugin in the pull requests and are able to update to a new version yourself - please visit [this page](https://shop.blackbit.de/de/service-xt-commerce/bitbucket-zugriff-xt-commerce-plugin-entwicklung) if this sounds interesting to you - if it does, please send us the email address of your BitBucket account so we can allow access to the repository.

When we allow your account to access our repository, please add the repository to the `composer.json` in your Pimcore root folder (see [Composer repositories](https://getcomposer.org/doc/05-repositories.md#vcs)):
```json
"repositories": [
    {
        "type": "vcs",
        "url": "git@bitbucket.org:blackbitwerbung/pimcore-plugins-external-sitemaps"
    }
],
```

Alternatively if you received the plugin code as zip file, please upload the zip file to your server (e.g. to the Pimcore root folder) and add the following to your `composer.json`:
```json
"repositories": [
    {
        "type": "artifact",
        "url": "path/to/directory/with/zip-file/"
    }
]
```

Then you should be able to execute `composer require blackbit/external-sitemaps` (or `composer update blackbit/external-sitemaps --no-dev` for updates if you already have this bundle installed) from CLI.

At last you have to enable the plugin, either via browser UI in Pimcore admin or via CLI:

`bin/console pimcore:bundle:enable BlackbitExternalSitemapsBundle`


### Plugin configuration

To define the external sitemap URLs, you have to override the symfony service `Blackbit\ExternalSitemapsBundle\ExternalSitemapGenerator` in `config/services.yaml` (Pimcore >= 10) or `app/config/services.yml`(Pimcore <= 6).

```yaml
Blackbit\ExternalSitemapsBundle\ExternalSitemapGenerator:
    arguments:
        $externalUrls: [ 'https://example.org/sitemap.xml', 'https://example2.org/sitemapIndex.xml' ]
```

After configuration is complete all external sitemap URLs will be put into `sitemap.externalUrls.xml` in your default Pimcore sitemaps index `/sitemap.xml` file.