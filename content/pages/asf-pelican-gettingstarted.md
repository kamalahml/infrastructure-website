Title: ASF-Pelican getting-started guide

Any ASF project using a Git repository for their website code and resources can use the [ASF-Pelican](asf-pelican.html) as the basis for their project website. 

Ensure that your site satisfies the ASF's <a href="https://infra.apache.org/project-site.html" target="_blank">guidelines for project websites</a>.


  1. Using <a href="https://selfserve.apache.org/" target="_blank">self-serve</a>, create a new repo for the code and resources for your project’s website.
  2. Clone the empty repo to a location on your computer.
  3. Use [Pelican's getting started guide](https://docs.getpelican.com/en/3.1.1/getting_started.html#kickstart-a-blog) to create a website in your repo or use the provided [template](https://github.com/apache/template-site)
  5. Configure [.asf.yaml](asf-yaml.html).

```
staging:
  profile: ~
  whoami: YOUR SITE'S GENERATED CONTENT BRANCH
  autostage: preview/*
```

  6. Configure <a href="https://infra.apache.org/asf-pelican-config.html" target="_blank">pelicanconf.py</a>.
  7. Use the Infrastructure provided [GitHub Actions workflow](https://github.com/apache/infrastructure-actions/raw/main/pelican/migration/build-pelican.yml) and ensure that the workflow shows the correct branches.
  8. Commit and push your new website repository. This should trigger the automatic build to staging (`REPONAME.staged.apache.org`).
  9. Review the site to confirm that the template materials display and function correctly.

### Using the Template

If you've opted to use the template to create your pelican site, you can follow these instructions:
  1. Download the [template](https://github.com/apache/template-site/archive/refs/heads/main.zip)
  2. Unzip the contents into your directory.
  3. Add your own content, updating, replacing, and removing template content elements as appropriate. With each commit / push of content, visit the staging site to confirm that the site displays as you expect it to.
     - `.md` files support GitHub Flavored Markdown ([**gfm**](gfm.html)) and html.
     - `.ezmd` files are for templates using `ASF_DATA`. .ezmd is a markdown extension of <a href="https://github.com/gstein/ezt/blob/wiki/Syntax.md" target="_blank">EZT</a>. It lets you embed ezt inside markdown with modifications to simplify the process of fetching generated/external data.
  4. <a href="https://infra.apache.org/asf-pelican-theme.html" target="_blank">Adjust the theme</a> by editing `base.html` and making any other style changes that will help the site present your project and product well. Don't forget to provide your product's logo in the `content/images` folder.
  5. When you are ready to publish the site, create a pull request to merge the content in staging into the trunk of the repo. That will trigger a build of the live site.
  6. Visit `YourProject.apache.org` after every update to make sure it displays and functions correctly.

**Note**: we strongly suggest that you do your site development in a [branch](apache-pelican-branches.html) rather than the trunk of the repository, and then merge the branch into the trunk when you are sure that everything is working as you would like it. Each commit to the trunk triggers an automatic build to update your live site; this is great for trivial changes like correcting typos, but more of a challenge if you are making major changes and it turns out that there is an error in your code that disables your live site. 

### Frameworks

The example has the following frameworks.

     - JavaScript:
       - [JQuery 3.6.0 Slim](https://code.jquery.com/jquery-3.6.0.slim.js)
       - [Popper 1.14.7](https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.js)
       - [Bootstrap 4.3.1](https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.js)
     - CSS:
       - [Bootstrap 4.3.1](https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.css)
       - [GitHub Markdown 3.0.1](https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/3.0.1/github-markdown.css)

For fenced code highlighting, consider <a href="https://highlightjs.org" target="_blank">highlightjs</a>.

### Data model

Determine whether your site requires a [data model](asf-pelican-data.html).

The `.ezmd` files in the template's `content` directory show examples, and <a href="https://github.com/apache/template-site/blob/main/asfdata.yaml" target="_blank">asfdata.yaml</a> has many examples.

Remove the following if you do not need a data model:
  - `asfdata.yaml`
  - `data/eccn` directory

## Issues and template questions

Please let us know if you run into [issues](https://github.com/apache/template-site/issues) with the template.

## Earlier versions

Earlier versions of this template made use of a `pelicanconf.py` configuration file. The current version uses `.asf.yaml` and `pelicanconf.yaml`, as noted above. We retain the earlier instruction for the projects using the earlier version of the template; however, any project starting with the template now should use the files and instructions noted above.

```
 Edit the `pelicanconf.py` configuration file:

   - Website specific
   - `PLUGINS`
   - `ASF_DATA` - `asfdata.py` plugin settings
   - `ASF_GENID` - `asfgenid.py` plugin settings
     `asfgenid.py` performs a series of html fixups including permalinks, heading ids, and table of contents
```
