# Vue Lunch & Learn

## Part 05 - Publish to Netlify (and set up CD)

### Instructions

* Continue editing `index.html`

* Prepare for deployment, switch to the production version of Vue

```html
<!-- production version, optimized for size and speed -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

* Initialize a git repo

```
echo "# vue-js-lunch-learn-test01" >> README.md
git init
git add .
git commit -m "first commit"
```

* Sign in to Github
* Create a new repository
* Generate a new Personal access token in Github - Settings - Developer Settings

* Push everything to master

```
git remote add origin https://github.com/kiley0/vue-js-lunch-learn-test01.git
git push -u origin master
```

### Set up continuous deployment

* Go to https://www.netlify.com/
* Create a new site from github

- Try the site after it publishes, notice a bug (no https)
- Fix https in BOTH fetch requests

```
git add .
git commit -m "fixed https"
git push -u -origin master
```

* Watch as it auto deploys when commit to master

* Done! HTTPS, continuous deployment, hosted on global CDN
* Tiny download size (see network tab)
* Excellent Lighthous scores (see audit tab)
